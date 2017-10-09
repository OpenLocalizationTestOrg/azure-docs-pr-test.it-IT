---
title: impostazioni del cluster di Azure Service Fabric aaaChange | Documenti Microsoft
description: "Questo articolo descrive le impostazioni dell'infrastruttura di hello e hello infrastruttura aggiornamento criteri che è possibile personalizzare."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Personalizzare le impostazioni del cluster Service Fabric e dei criteri di aggiornamento dell'infrastruttura
Questo documento indica la modalità toocustomize hello diverse impostazioni di infrastruttura e i criteri di aggiornamento dell'infrastruttura hello per il cluster di Service Fabric. È possibile personalizzarle nel portale di hello o tramite un modello di gestione risorse di Azure.

> [!NOTE]
> Non tutte le impostazioni possono essere disponibili tramite il portale di hello. Nel caso in cui un'impostazione elencata di seguito non è disponibile tramite il portale di hello personalizzarlo utilizzando un modello di gestione risorse di Azure.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Personalizzazione delle impostazioni del cluster di Service Fabric mediante modelli di Azure Resource Manager
Hello i passaggi seguenti illustrano come una nuova impostazione tooadd *MaxDiskQuotaInMB* toohello *diagnostica* sezione.

1. Passare toohttps://resources.azure.com
2. Passare a sottoscrizione tooyour espandendo sottoscrizioni -> risorse -> gruppi Microsoft.ServiceFabric -> il nome del Cluster
3. In hello angolo superiore destro, selezionare "In lettura/scrittura"
4. Selezionare Modifica e aggiornamento hello `fabricSettings` elemento JSON e aggiungere un nuovo elemento

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Impostazioni di infrastruttura che è possibile personalizzare
Ecco le impostazioni dell'infrastruttura di hello che è possibile personalizzare:

### <a name="section-name-diagnostics"></a>Nome della sezione: Diagnostics
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ConsumerInstances |String |elenco di Hello delle istanze di consumer DCA. |
| ProducerInstances |String |elenco di Hello delle istanze di producer DCA. |
| AppEtwTraceDeletionAgeInDays |Int, valore predefinito: 3 |Il numero di giorni dopo il quale i file ETL meno recenti contenenti tracce ETW di applicazioni vengono eliminati. |
| AppDiagnosticStoreAccessRequiresImpersonation |Bool, valore predefinito: true |Se la rappresentazione è obbligatoria quando l'accesso a diagnostica archiviato per conto di un'applicazione hello. |
| MaxDiskQuotaInMB |Int, valore predefinito: 65536 |Quota del disco in MB per i file di log di Windows Fabric. |
| DiskFullSafetySpaceInMB |Int, valore predefinito: 1024 |Spazio su disco rimanente in MB tooprotect dall'utilizzo in DCA. |
| ApplicationLogsFormatVersion |Int, valore predefinito: 0 |Versione per il formato dei log applicazioni. I valori supportati sono 0 e 1. Versione 1 include più campi di record di eventi ETW di hello versione 0. |
| ClusterId |String |id univoco di Hello del cluster di hello. Viene generato quando viene creato il cluster hello. |
| EnableTelemetry |Bool, valore predefinito: true |Questo accade tooenable o disabilitare i dati di telemetria. |
| EnableCircularTraceSession |Bool, valore predefinito: false |Il flag indica se devono essere usate le sessioni di traccia circolari. |

### <a name="section-name-traceetw"></a>Nome della sezione: Trace/Etw
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| Level |Int, valore predefinito: 4 |Il livello di traccia ETW può accettare valori 1, 2, 3 e 4. toobe supportata è necessario mantenere il livello di traccia hello 4 |

### <a name="section-name-performancecounterlocalstore"></a>Nome della sezione: PerformanceCounterLocalStore
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| IsEnabled |Bool, valore predefinito: true |Il flag indica se è abilitata la raccolta dei contatori delle prestazioni nel nodo locale. |
| SamplingIntervalInSeconds |Int, valore predefinito: 60 |Intervallo di campionamento per i contatori delle prestazioni che vengono raccolti. |
| Counters |String |Elenco delimitato da virgole di toocollect i contatori delle prestazioni. |
| MaxCounterBinaryFileSizeInMB |Int, valore predefinito: 1 |Dimensione massima (in MB) per ogni file binario del contatore delle prestazioni. |
| NewCounterBinaryFileCreationIntervalInMinutes |Int, valore predefinito: 10 |Intervallo massimo (in secondi) dopo il quale viene creato un nuovo file binario di contatore delle prestazioni. |

### <a name="section-name-setup"></a>Nome della sezione: Setup
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| FabricDataRoot |string |La directory radice dei dati di Service Fabric. L'impostazione predefinita per Azure è d:\svcfab |
| FabricLogRoot |string |La directory radice dei log di Service Fabric. Si tratta della posizione in cui vengono collocate le tracce e i log di Service Fabric. |
| ServiceRunAsAccountName |String |nome dell'account Hello in quale servizio host di fabric toorun. |
| ServiceStartupType |String |tipo di avvio Hello del servizio host di fabric hello. |
| SkipFirewallConfiguration |Bool, valore predefinito: false |Specifica se le impostazioni del firewall necessario toobe impostato dal sistema hello o meno. Si applica solo se si usa Windows Firewall. Se si utilizza il firewall di terze parti, è necessario aprire porte hello per hello toouse di sistema e delle applicazioni |

### <a name="section-name-transactionalreplicator"></a>Nome della sezione: TransactionalReplicator
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| MaxCopyQueueSize |Uint, valore predefinito: 16384 |Si tratta di valore massimo hello definisce le dimensioni iniziali hello per coda hello che gestisce le operazioni di replica. Si noti che deve essere una potenza di 2. Se durante il runtime hello coda cresce operazioni dimensioni toothis verranno limitate tra Replicator di hello primario e secondario. |
| BatchAcknowledgementInterval | Tempo in secondi, valore predefinito: 0,015 | Specificare l'intervallo di tempo in secondi. Determina hello quantità di tempo che hello attese replicator dopo la ricezione di un'operazione prima dell'invio di un riconoscimento. Altre operazioni ricevuti durante questo periodo di tempo avrà i relativi riconoscimenti inviati di nuovo in un singolo messaggio -> riducendo il traffico di rete ma potenzialmente riduzione della velocità effettiva hello di replicator hello. |
| MaxReplicationMessageSize |Uint, valore predefinito: 52428800 | Dimensioni massime dei messaggi delle operazioni di replica. Il valore predefinito è 50 MB. |
| ReplicatorAddress |stringa, il valore predefinito è "localhost:0" | endpoint di Hello in forma di stringa-'Creato' usato dalle connessioni tooestablish di Windows Fabric Replicator hello con altre repliche nelle operazioni toosend/ricezione dell'ordine. |
| InitialPrimaryReplicationQueueSize |Uint, valore predefinito: 64 | Questo valore definisce le dimensioni iniziali hello per coda hello che gestisce le operazioni di replica hello in hello primario. Si noti che deve essere una potenza di 2.|
| MaxPrimaryReplicationQueueSize |Uint, valore predefinito: 8192 |Si tratta hello il numero massimo di operazioni che possono essere presenti nella coda di replica primaria hello. Si noti che deve essere una potenza di 2. |
| MaxPrimaryReplicationQueueMemorySize |Uint, valore predefinito: 0 |Questo è hello valore massimo della coda di replica primaria hello in byte. |
| InitialSecondaryReplicationQueueSize |Uint, valore predefinito: 64 |Questo valore definisce le dimensioni iniziali hello per coda hello che gestisce le operazioni di replica hello in hello secondario. Si noti che deve essere una potenza di 2. |
| MaxSecondaryReplicationQueueSize |Uint, valore predefinito: 16384 |Si tratta hello il numero massimo di operazioni che possono essere presenti nella coda di replica secondaria hello. Si noti che deve essere una potenza di 2. |
| MaxSecondaryReplicationQueueMemorySize |Uint, valore predefinito: 0 |Questo è hello valore massimo della coda di replica secondaria hello in byte. |
| SecondaryClearAcknowledgedOperations |Bool, valore predefinito: false |Bool che controlla se le operazioni di hello nella replica secondaria hello vengono cancellate dopo che vengano riconosciuti toohello primario (toohello scaricato su disco). Impostazioni in che può causare questo tooTRUE letture disco aggiuntivo hello nuovo database primario, mentre recuperando le repliche dopo un failover. |
| MaxMetadataSizeInKB |Int, valore predefinito: 4 |Dimensione massima del flusso dei metadati del Registro di hello. |
| MaxRecordSizeInKB |Uint, valore predefinito: 1024 | Dimensione massima del record di un flusso di log. |
| CheckpointThresholdInMB |Int, valore predefinito: 50 |Verrà avviato un checkpoint quando l'utilizzo di log hello supera questo valore. |
| MaxAccumulatedBackupLogSizeInMB |Int, valore predefinito: 800 |Dimensioni massime accumulate (in MB) dei log di backup in una data catena di log di backup. Un richieste backup incrementale avrà esito negativo se il backup incrementale hello genererebbe un backup del log che provocherebbero hello accumulato backup log perché hello rilevanti backup completo toobe più grande della dimensione. In questi casi, l'utente è obbligatorio tootake un backup completo. |
| MaxWriteQueueDepthInKB |Int, valore predefinito: 0 | Int per massimo profondità della coda di scrittura logger core hello è possibile utilizzare come specificato in kilobyte di log hello associata a questa replica. Questo valore è numero massimo di hello di byte che possono essere in sospeso durante gli aggiornamenti di logger di base. Può essere 0 per hello core logger toocompute un valore appropriato o un multiplo di 4. |
| SharedLogId |String |Identificatore di un log condiviso. È un valore GUID e deve essere univoco per ciascun log condiviso. |
| SharedLogPath |String |Log condiviso toohello percorso. Se questo valore è vuoto, quindi hello log condivisa viene utilizzata l'impostazione predefinita. |
| SlowApiMonitoringDuration |Tempo in secondi, il valore predefinito è 300 | Specificare la durata per l'API prima che venga generato l'evento di integrità dell'avviso.|
| MinLogSizeInMB |Int, valore predefinito: 0 |Dimensioni minime del log delle transazioni hello. log Hello non potrà essere tootruncate tooa dimensioni di sotto di questa impostazione. 0 indica che replicator hello determinerà hello dimensione minima del registro in base a impostazioni tooother. Aumentando questo valore aumenta hello possibilità copie parziali e i backup incrementali dal possibilità di record del log rilevanti è ridotto il troncamento. |

### <a name="section-name-fabricclient"></a>Nome della sezione: FabricClient
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| NodeAddresses |stringa, il valore predefinito è "" |Raccolta di indirizzi (le stringhe di connessione) in nodi diversi che possono essere utilizzati toocommunicate con hello hello Naming Service. Inizialmente hello che client si connette la selezione di uno degli indirizzi hello in modo casuale. Se viene specificata più di una stringa di connessione e una connessione non riesce a causa di una comunicazione o un errore di timeout. Hello Client passa successivo indirizzo di toouse hello in sequenza. Hello indirizzo del servizio di denominazione tentativi per vedere i dettagli sulla semantica di tentativi. |
| ConnectionInitializationTimeout |Tempo in secondi, valore predefinito: 2 |Specificare l'intervallo di tempo in secondi. Intervallo di timeout di connessione per ogni client in fase di prova tooopen un gateway di connessione toohello. |
| PartitionLocationCacheLimit |Int, valore predefinito: 100000 |Numero di partizioni nella cache per la risoluzione di servizio (set too0 indica nessun limite). |
| ServiceChangePollInterval |Tempo in secondi, valore predefinito: 120 |Specificare l'intervallo di tempo in secondi. intervallo di Hello tra i polling consecutivi per il servizio cambia da gateway di toohello hello client per i callback di notifiche di modifica di servizio registrato. |
| KeepAliveIntervalInSeconds |Int, valore predefinito: 20 |intervallo di Hello quali hello FabricClient trasporto invia gateway toohello messaggi keep-alive. Se il valore è 0, keepAlive è disabilitato. Deve essere un valore positivo. |
| HealthOperationTimeout |Tempo in secondi, valore predefinito: 120 |Specificare l'intervallo di tempo in secondi. timeout di Hello per un messaggio di rapporto inviato tooHealth Manager. |
| HealthReportSendInterval |Tempo in secondi, il valore predefinito è 30 |Specificare l'intervallo di tempo in secondi. intervallo di Hello alla quale componente di report Invia accumulato integrità segnala tooHealth Manager. |
| HealthReportRetrySendInterval |Tempo in secondi, il valore predefinito è 30 |Specificare l'intervallo di tempo in secondi. intervallo di Hello alla quale componente di report invia nuovamente accumulato integrità segnala tooHealth Manager. |
| RetryBackoffInterval |Tempo in secondi, valore predefinito: 3 |Specificare l'intervallo di tempo in secondi. Hello intervallo di Backoff prima di ritentare l'operazione di hello. |
| MaxFileSenderThreads |Uint, valore predefinito: 10 |Numero max di Hello di file che vengono trasferiti in parallelo. |

### <a name="section-name-common"></a>Nome della sezione: Common
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| PerfMonitorInterval |Tempo in secondi, valore predefinito: 1 |Specificare l'intervallo di tempo in secondi. Intervallo del monitoraggio delle prestazioni. Impostazione too0 o un valore negativo disattiva il monitoraggio. |

### <a name="section-name-healthmanager"></a>Nome della sezione: HealthManager
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |Bool, valore predefinito: false |Criteri di valutazione dell'integrità del cluster: abilitare il parametro per la valutazione dell'integrità del tipo di applicazione. |

### <a name="section-name-fabricnode"></a>Nome della sezione: FabricNode
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| StateTraceInterval |Tempo in secondi, il valore predefinito è 300 |Specificare l'intervallo di tempo in secondi. intervallo di Hello per tenere traccia dello stato di nodo in ogni nodo e dei nodi in FM/FMM. |

### <a name="section-name-nodedomainids"></a>Nome della sezione: NodeDomainIds
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| UpgradeDomainId |stringa, il valore predefinito è "" |Viene descritto il dominio di aggiornamento hello che appartiene a un nodo. |
| PropertyGroup |NodeFaultDomainIdCollection |Descrive i domini di errore hello che appartiene a un nodo. dominio di errore Hello è definito tramite un URI che descrive il percorso di hello del nodo hello in Data Center hello.  URI di domini di errore sono di hello formattare fd: / fd/seguita da un segmento di percorso URI.|

### <a name="section-name-nodeproperties"></a>Nome della sezione: NodeProperties
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Una raccolta di coppie di stringhe chiave-valore per le proprietà del nodo. |

### <a name="section-name-nodecapacities"></a>Nome della sezione: NodeCapacities
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Una raccolta di capacità dei nodi per diverse metriche. |

### <a name="section-name-fabricnode"></a>Nome della sezione: FabricNode
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| StartApplicationPortRange |Int, valore predefinito: 0 |Avvio delle porte applicazione hello gestiti dal sottosistema di hosting. Obbligatorio se EndpointFilteringEnabled è impostato su true in Hosting. |
| EndApplicationPortRange |Int, valore predefinito: 0 |End (non inclusivo) delle porte applicazione hello gestiti dal sottosistema di hosting. Obbligatorio se EndpointFilteringEnabled è impostato su true in Hosting. |
| ClusterX509StoreName |stringa, il valore predefinito è "My" |Nome dell'archivio certificati X.509 che contiene il certificato del cluster per proteggere la comunicazione all'interno del cluster. |
| ClusterX509FindType |stringa, valore predefinito è "FindByThumbprint" |Indica come toosearch per il certificato del cluster nell'archivio di hello specificato dai valori ClusterX509StoreName supportato: "FindByThumbprint"; "FindBySubjectName" con "FindBySubjectName"; Quando sono presenti più corrispondenze; Hello con scadenza più lontana hello viene utilizzato. |
| ClusterX509FindValue |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato di cluster. |
| ClusterX509FindValueSecondary |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato di cluster. |
| ServerAuthX509StoreName |stringa, il valore predefinito è "My" |Nome dell'archivio certificati X.509 che contiene il certificato server per il servizio di entrata. |
| ServerAuthX509FindType |stringa, valore predefinito è "FindByThumbprint" |Indica come toosearch per certificato server nell'archivio di hello specificato dal valore ServerAuthX509StoreName supportati: FindByThumbprint; FindBySubjectName. |
| ServerAuthX509FindValue |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato del server. |
| ServerAuthX509FindValueSecondary |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato del server. |
| ClientAuthX509StoreName |stringa, il valore predefinito è "My" |Nome dell'archivio di certificati x. 509 hello che contiene un certificato per il ruolo di amministratore predefinito FabricClient. |
| ClientAuthX509FindType |stringa, valore predefinito è "FindByThumbprint" |Indica come toosearch per il certificato nell'archivio di hello specificato dal valore ClientAuthX509StoreName supportati: FindByThumbprint; FindBySubjectName. |
| ClientAuthX509FindValue |stringa, il valore predefinito è "" | Il valore di filtro di ricerca utilizzato toolocate certificato per il ruolo di amministratore predefinito FabricClient. |
| ClientAuthX509FindValueSecondary |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato per il ruolo di amministratore predefinito FabricClient. |
| UserRoleClientX509StoreName |stringa, il valore predefinito è "My" |Nome dell'archivio di certificati x. 509 hello che contiene un certificato per il ruolo utente predefinito FabricClient. |
| UserRoleClientX509FindType |stringa, valore predefinito è "FindByThumbprint" |Indica come toosearch per il certificato nell'archivio di hello specificato dal valore UserRoleClientX509StoreName supportati: FindByThumbprint; FindBySubjectName. |
| UserRoleClientX509FindValue |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato per il ruolo utente predefinito FabricClient. |
| UserRoleClientX509FindValueSecondary |stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato toolocate certificato per il ruolo utente predefinito FabricClient. |

### <a name="section-name-paas"></a>Nome della sezione: Paas
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ClusterId |stringa, il valore predefinito è "" |Archivio certificati X.509 usato da Service Fabric per la protezione della configurazione. |

### <a name="section-name-fabrichost"></a>Nome della sezione: FabricHost
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| StopTimeout |Tempo in secondi, il valore predefinito è 300 |Specificare l'intervallo di tempo in secondi. timeout per l'attivazione del servizio ospitato; Hello la disattivazione e l'aggiornamento. |
| StartTimeout |Tempo in secondi, il valore predefinito è 300 |Specificare l'intervallo di tempo in secondi. Timeout per l'avvio di fabricactivationmanager. |
| ActivationRetryBackoffInterval |Tempo in secondi, valore predefinito: 5 |Specificare l'intervallo di tempo in secondi. Intervallo di Backoff in ogni caso di errore di attivazione; ogni attivazione continua sistema hello errore eseguirà un nuovo tentativo attivazione hello per backup toohello MaxActivationFailureCount. intervallo tra tentativi Hello ogni tentativo è un prodotto di attivazione continua errore e hello Backoff intervallo di attivazione. |
| ActivationMaxRetryInterval |Tempo in secondi, il valore predefinito è 300 |Specificare l'intervallo di tempo in secondi. Intervallo massimo tra i tentativi di attivazione. In ogni tentativo di hello continua intervallo viene calcolato come Min (ActivationMaxRetryInterval; Numero di errori continui * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Int, valore predefinito: 10 |Questo è il numero massimo di hello per il quale sistema eseguirà un nuovo tentativo attivazione non riuscita prima di rinunciare. |
| EnableServiceFabricAutomaticUpdates |Bool, valore predefinito: false |Si tratta di aggiornamenti automatici di infrastruttura tooenable tramite Windows Update. |
| EnableServiceFabricBaseUpgrade |Bool, valore predefinito: false |Questo è tooenable aggiornamento di base per server. |
| EnableRestartManagement |Bool, valore predefinito: false |Si tratta di tooenable riavvio del server. |


### <a name="section-name-failovermanager"></a>Nome della sezione: FailoverManager
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Tempo in secondi, valore predefinito: 60,0 * 30 |Specificare l'intervallo di tempo in secondi. Quando una replica persistente arresta; Windows Fabric attende che la durata per hello replica toocome eseguire il backup prima di creare nuove repliche di sostituzione (che richiedono una copia dello stato di hello). |
| QuorumLossWaitDuration |Tempo in secondi, valore predefinito: MaxValue |Specificare l'intervallo di tempo in secondi. Si tratta di durata massima di hello per cui è consentito toobe una partizione in uno stato di perdita del quorum. Se la partizione hello è ancora in perdita del quorum dopo questa durata; partizione Hello verrà ripristinati dalla perdita di quorum prendendo in considerazione hello verso il basso le repliche come persa. Ciò può comportare una potenziale perdita di dati. |
| UserStandByReplicaKeepDuration |Tempo in secondi, il valore predefinito è 3600.0 * 24 * 7 |Specificare l'intervallo di tempo in secondi. Quando una replica persistente torna online, potrebbe già essere stata sostituita. Questo timer determina quanto tempo hello FM manterrà replica standby hello prima di rimuoverli. |
| UserMaxStandByReplicaCount |Int, valore predefinito: 1 |numero massimo predefinito di Hello di repliche StandBy che consente di mantenere sistema hello per i servizi utente. |

### <a name="section-name-namingservice"></a>Nome della sezione: NamingService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, valore predefinito: 7 |numero di Hello di replica imposta per ogni partizione dell'archivio di hello Naming Service. Aumentare il numero di hello replica set aumenta hello livello di affidabilità per le informazioni di hello nell'archivio del servizio di denominazione; hello diminuendo modifica hello hello informazioni andranno persi in seguito a errori di nodo. al costo di un carico maggiore sul Windows Fabric e hello tempo impiegato aggiornamenti tooperform toohello denominazione dei dati.|
|MinReplicaSetSize | Int, valore predefinito: 3 | numero minimo di Hello delle repliche Naming Service necessari toowrite in toocomplete un aggiornamento. Se sono presenti repliche di un numero inferiore rispetto a questo attive in hello sistema hello affidabilità sistema Nega l'archivio del servizio di denominazione toohello aggiornamenti fino a quando non vengono ripristinate le repliche. Questo valore non deve essere mai più di hello TargetReplicaSetSize. |
|ReplicaRestartWaitDuration | Tempo in secondi, valore predefinito: (60.0 * 30)| Specificare l'intervallo di tempo in secondi. Quando una replica di Naming Service si arresta, si avvia questo timer.  Scadenza hello FM inizierà tooreplace hello repliche verso il basso (non ancora considera li perse). |
|QuorumLossWaitDuration | Tempo in secondi, valore predefinito: MaxValue | Specificare l'intervallo di tempo in secondi. Quando un Naming Service entra in uno stato di perdita del quorum, si avvia questo timer.  Scadenza hello FM considererà hello verso il basso le repliche andrà persa. e tentare di toorecover quorum. Questa azione può comportare la perdita di dati. |
|StandByReplicaKeepDuration | Tempo in secondi, valore predefinito: è 3600.0 * 2 | Specificare l'intervallo di tempo in secondi. Quando un Naming Service torna online, potrebbe già essere stata sostituito.  Questo timer determina quanto tempo hello FM manterrà replica standby hello prima di rimuoverli. |
|PlacementConstraints | stringa, il valore predefinito è "" | Vincoli di posizionamento per hello Naming Service. |
|ServiceDescriptionCacheLimit | Int, valore predefinito: 0 | numero massimo di Hello di voci contenute nella cache di hello LRU servizio descrizione a hello denominazione il servizio di archiviazione (set too0 indica nessun limite). |
|RepairInterval | Tempo in secondi, valore predefinito: 5 | Specificare l'intervallo di tempo in secondi. Intervallo nel quale hello inizierà denominazione riparazione di un'incoerenza tra hello autorità proprietario principale e nome. |
|MaxNamingServiceHealthReports | Int, valore predefinito: 10 | numero massimo di Hello di operazioni lente che denominazione archiviare report non integro del servizio in una sola volta. Se il valore è 0, verranno incluse tutte le operazioni lente. |
| MaxMessageSize |Int, valore predefinito: 4*1024*1024 |dimensione massima del messaggio Hello per le comunicazioni di nodo client quando si utilizza di denominazione. Attenuazione di attacchi DOS, valore predefinito: 4 MB. |
| MaxFileOperationTimeout |Tempo in secondi, il valore predefinito è 30 |Specificare l'intervallo di tempo in secondi. Hello timeout massimo consentito per l'operazione di servizio di archivio file. Le richieste che specificano un timeout maggiore verranno respinte. |
| MaxOperationTimeout |Tempo in secondi, valore predefinito: 600 |Specificare l'intervallo di tempo in secondi. Hello timeout massimo consentito per le operazioni dei client. Le richieste che specificano un timeout maggiore verranno respinte. |
| MaxClientConnections |Int, valore predefinito: 1000 |Hello numero massimo consentito di connessioni client al gateway. |
| ServiceNotificationTimeout |Tempo in secondi, il valore predefinito è 30 |Specificare l'intervallo di tempo in secondi. timeout di Hello utilizzato per la consegna client toohello notifiche del servizio. |
| MaxOutstandingNotificationsPerClient |Int, valore predefinito: 1000 |numero massimo di Hello di notifiche in sospeso prima di una registrazione di client viene chiusa forzatamente dal gateway hello. |
| MaxIndexedEmptyPartitions |Int, valore predefinito: 1000 |numero massimo di Hello di partizioni vuote che rimarrà indicizzato nella cache di hello notifica per la sincronizzazione client la riconnessione. Le partizioni vuote di sopra di questo numero verranno rimossa dall'indice hello in senso crescente della versione di ricerca. Riconnessione dei client possono essere ancora sincronizzate e ricevere gli aggiornamenti mancanti partizione vuota. ma il protocollo di sincronizzazione hello diventa più costoso. |
| GatewayServiceDescriptionCacheLimit |Int, valore predefinito: 0 |numero massimo di Hello di voci contenute nella cache di hello LRU servizio descrizione a hello Naming Gateway (set too0 indica nessun limite). |
| PartitionCount |Int, valore predefinito: 3 |numero di Hello delle partizioni di hello Naming Service archivio toobe creato. Ogni partizione possiede una chiave singola partizione corrispondente indice tooits; chiavi di partizione in questo caso [0; PartitionCount) esiste. Imposta numero crescente di hello di partizioni Naming Service scala hello hello Naming Service può eseguire in riducendo il tempo medio di hello di dati mantenuti da qualsiasi replica di backup. a un costo maggiore utilizzo delle risorse (poiché PartitionCount * è necessario configurare le repliche del servizio ReplicaSetSize).|

### <a name="section-name-runas"></a>Nome della sezione: RunAs
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| RunAsAccountName |stringa, il valore predefinito è "" |Indica hello nome dell'account RunAs. Parametro necessario solo per i tipi di account "DomainUser" o "ManagedServiceAccount". I valori validi sono "dominio\utente" o "user@domain". |
|RunAsAccountType|stringa, il valore predefinito è "" |Indica i tipo di account RunAs hello. Parametro necessario per ogni sezione RunAs. I valori validi sono: "DomainUser/NetworkService/ManagedServiceAccount/LocalSystem".|
|RunAsPassword|stringa, il valore predefinito è "" |Indica la password di account RunAs hello. Parametro necessario solo per il tipo di account "DomainUser". |

### <a name="section-name-runasfabric"></a>Nome della sezione: RunAs_Fabric
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| RunAsAccountName |stringa, il valore predefinito è "" |Indica hello nome dell'account RunAs. Parametro necessario solo per i tipi di account "DomainUser" o "ManagedServiceAccount". I valori validi sono "dominio\utente" o "user@domain". |
|RunAsAccountType|stringa, il valore predefinito è "" |Indica i tipo di account RunAs hello. Parametro necessario per ogni sezione RunAs. I valori validi sono: "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|stringa, il valore predefinito è "" |Indica la password di account RunAs hello. Parametro necessario solo per il tipo di account "DomainUser". |

### <a name="section-name-runashttpgateway"></a>Nome della sezione: RunAs_HttpGateway
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| RunAsAccountName |stringa, il valore predefinito è "" |Indica hello nome dell'account RunAs. Parametro necessario solo per i tipi di account "DomainUser" o "ManagedServiceAccount". I valori validi sono "dominio\utente" o "user@domain". |
|RunAsAccountType|stringa, il valore predefinito è "" |Indica i tipo di account RunAs hello. Parametro necessario per ogni sezione RunAs. I valori validi sono: "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|stringa, il valore predefinito è "" |Indica la password di account RunAs hello. Parametro necessario solo per il tipo di account "DomainUser". |

### <a name="section-name-runasdca"></a>Nome della sezione: RunAs_DCA
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| RunAsAccountName |stringa, il valore predefinito è "" |Indica hello nome dell'account RunAs. Parametro necessario solo per i tipi di account "DomainUser" o "ManagedServiceAccount". I valori validi sono "dominio\utente" o "user@domain". |
|RunAsAccountType|stringa, il valore predefinito è "" |Indica i tipo di account RunAs hello. Parametro necessario per ogni sezione RunAs. I valori validi sono: "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|stringa, il valore predefinito è "" |Indica la password di account RunAs hello. Parametro necessario solo per il tipo di account "DomainUser". |

### <a name="section-name-httpgateway"></a>Nome della sezione: HttpGateway
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
|IsEnabled|Bool, valore predefinito: false | Abilita o disabilita hello httpgateway. Httpgateway è disabilitato per impostazione predefinita e questa configurazione deve toobe set tooenable è. |
|ActiveListeners |Uint, valore predefinito: 50 | Numero di operazioni di lettura coda del server http toohello toopost. Controlla il numero di hello di richieste simultanee che possono essere soddisfatti da hello HttpGateway. |
|MaxEntityBodySize |Uint, valore predefinito: 4194304 |  Fornisce dimensioni massime di hello del corpo hello che è possibile prevedere una richiesta http. Il valore predefinito è 4 MB. Httpgateway non porterà a termine una richiesta se questa ha un corpo di dimensioni superiori al valore indicato. La dimensione minima dei blocchi di lettura è di 4096 byte. In modo ha toobe > = 4096. |
|HttpGatewayHealthReportSendInterval |Tempo in secondi, il valore predefinito è 30 | Specificare l'intervallo di tempo in secondi. intervallo di Hello quali hello Http Gateway invia accumulati tooHealth rapporti di integrità Manager. |

### <a name="section-name-ktllogger"></a>Nome della sezione: KtlLogger
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Int, valore predefinito: 1 | Flag che indica se le impostazioni della memoria hello devono configurate automaticamente e in modo dinamico. Se le impostazioni di configurazione zero quindi hello memoria vengono utilizzate direttamente e non cambiano in base alle condizioni di sistema. Se una memoria hello impostazioni vengono configurate automaticamente e possono cambiare in base alle condizioni di sistema. |
|WriteBufferMemoryPoolMinimumInKB |Int, valore predefinito: 8388608 |numero di Hello di KB tooinitially allocare per il pool di memoria buffer di scrittura hello. Utilizzare 0 tooindicate alcun limite predefinito non dovrebbe essere coerente con SharedLogSizeInMB riportato di seguito. |
|WriteBufferMemoryPoolMaximumInKB | Int, valore predefinito: 0 |numero di Hello di hello tooallow KB scrittura toogrow di pool di buffer memoria fino a. Non usare 0 tooindicate alcun limite. |
|MaximumDestagingWriteOutstandingInKB | Int, valore predefinito: 0 | numero di Hello di hello tooallow KB condiviso tooadvance log prima di quelli di log dedicato hello. Non usare 0 tooindicate alcun limite.
|SharedLogPath |stringa, il valore predefinito è "" | Percorso e il nome toolocation tooplace condivisa contenitore di log. Usare "" per indicare il percorso predefinito nella radice dati di Service Fabric. |
|SharedLogId |stringa, il valore predefinito è "" |GUID univoco per il contenitore di log condivisi. Usare "" se si usa il percorso predefinito nella radice dati di Service Fabric. |
|SharedLogSizeInMB |Int, valore predefinito: 8192 | numero di Hello di tooallocate MB nel contenitore di log condiviso hello. |

### <a name="section-name-applicationgatewayhttp"></a>Nome della sezione: ApplicationGateway/Http
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
|IsEnabled |Bool, valore predefinito: false | Abilita o disabilita hello HttpApplicationGateway. HttpApplicationGateway è disabilitato per impostazione predefinita e questa configurazione deve toobe set tooenable è. |
|NumberOfParallelOperations | Uint, valore predefinito: 5000 | Numero di operazioni di lettura coda del server http toohello toopost. Controlla il numero di hello di richieste simultanee che possono essere soddisfatti da hello HttpGateway. |
|DefaultHttpRequestTimeout |Tempo in secondi, Il valore predefinito è 120 |Specificare l'intervallo di tempo in secondi.  Consente di timeout della richiesta di hello predefinito per le richieste http hello in fase di elaborazione nel gateway di hello http app. |
|ResolveServiceBackoffInterval |Tempo in secondi, valore predefinito: 5 |Specificare l'intervallo di tempo in secondi.  Offre hello back-off l'intervallo predefinito prima di ripetere un'operazione di servizio di risoluzione non riuscita. |
|BodyChunkSize |Uint, valore predefinito: 16384 |  Fornisce hello dimensioni per hello blocco in byte usata corpo hello tooread. |
|GatewayAuthCredentialType |stringa, il valore predefinito è "None" | Indica il tipo di hello di toouse le credenziali di sicurezza in hello http app gateway endpoint validi sono "None / X. 509. |
|GatewayX509CertificateStoreName |stringa, il valore predefinito è "My" | Nome dell'archivio certificati X.509 che contiene il certificato per il gateway applicazione http. |
|GatewayX509CertificateFindType |stringa, valore predefinito è "FindByThumbprint" | Indica come toosearch per il certificato nell'archivio di hello specificato dal valore GatewayX509CertificateStoreName supportati: FindByThumbprint; FindBySubjectName. |
|GatewayX509CertificateFindValue | stringa, il valore predefinito è "" | Il valore di filtro di ricerca utilizzato il certificato gateway toolocate hello http dell'app. Questo certificato è configurato nell'endpoint https hello e se può essere utilizzato tooverify hello identità dell'applicazione hello necessarie per i servizi di hello. Viene prima cercato FindValue. Se non esiste, viene cercato FindValueSecondary. |
|GatewayX509CertificateFindValueSecondary | stringa, il valore predefinito è "" |Il valore di filtro di ricerca utilizzato il certificato gateway toolocate hello http dell'app. Questo certificato è configurato nell'endpoint https hello e se può essere utilizzato tooverify hello identità dell'applicazione hello necessarie per i servizi di hello. Viene prima cercato FindValue. Se non esiste, viene cercato FindValueSecondary.|

### <a name="section-name-management"></a>Nome della sezione: Management
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | Toohello stringa di connessione principale per ImageStore. |
| ImageStoreMinimumTransferBPS | Int, valore predefinito: 1024 |velocità di trasferimento minimo Hello tra cluster hello e nell'archivio immagini. Questo valore è utilizzato toodetermine hello timeout durante l'accesso a hello nell'archivio di immagini esterna. Modificare questo valore solo se la latenza tra cluster hello e ImageStore hello è elevata tooallow più tempo per toodownload cluster hello da hello nell'archivio di immagini esterna. |
|AzureStorageMaxWorkerThreads | Int, valore predefinito: 25 | numero massimo di Hello di thread di lavoro in parallelo. |
|AzureStorageMaxConnections | Int, valore predefinito: 5000 | numero massimo di Hello di archiviazione tooazure connessioni simultanee. |
|AzureStorageOperationTimeout | Tempo in secondi, valore predefinito: 6000 | Specificare l'intervallo di tempo in secondi. Timeout per toocomplete operazione xstore. |
|ImageCachingEnabled | Bool, valore predefinito: true | Questa configurazione consente tooenable o disabilitare la memorizzazione nella cache. |
|DisableChecksumValidation | Bool, valore predefinito: false | Questa configurazione consente tooenable o disabilitare la convalida di checksum durante il provisioning dell'applicazione. |
|DisableServerSideCopy | Bool, valore predefinito: false | Questa configurazione Abilita o disabilita copia sul lato server del pacchetto dell'applicazione in ImageStore hello durante il provisioning dell'applicazione. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>Nome della sezione: HealthManager/ClusterHealthPolicy
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ConsiderWarningAsError |Bool, valore predefinito: false |Criteri di valutazione dell'integrità del cluster: gli avvisi vengano considerati come errori. |
| MaxPercentUnhealthyNodes | Int, valore predefinito: 0 |Criteri di valutazione di integrità del cluster: percentuale massima di nodi non integri consentita per hello cluster toobe integro. |
| MaxPercentUnhealthyApplications | Int, valore predefinito: 0 |Criteri di valutazione di integrità del cluster: percentuale massima di applicazioni non integre consentito per hello cluster toobe integro. |
|MaxPercentDeltaUnhealthyNodes | Int, valore predefinito: 10 |I criteri di valutazione dello stato di aggiornamento del cluster: percentuale massima di nodi non integri delta consentito per hello cluster toobe integro. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Int, valore predefinito: 15 |I criteri di valutazione dello stato di aggiornamento del cluster: delta di nodi non integri in un dominio di aggiornamento di percentuale massima consentita per hello cluster toobe integro.|

### <a name="section-name-faultanalysisservice"></a>Nome della sezione: FaultAnalysisService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, valore predefinito: 0 |Hello NOT_PLATFORM_UNIX_START TargetReplicaSetSize per FaultAnalysisService. |
| MinReplicaSetSize |Int, valore predefinito: 0 |Hello MinReplicaSetSize per FaultAnalysisService. |
| ReplicaRestartWaitDuration |Tempo in secondi, valore predefinito: 60 minuti|Specificare l'intervallo di tempo in secondi. Hello ReplicaRestartWaitDuration per FaultAnalysisService. |
| QuorumLossWaitDuration | Tempo in secondi, valore predefinito: MaxValue |Specificare l'intervallo di tempo in secondi. Hello QuorumLossWaitDuration per FaultAnalysisService. |
| StandByReplicaKeepDuration| Tempo in secondi, valore predefinito: (60*24*7) minuti |Specificare l'intervallo di tempo in secondi. Hello StandByReplicaKeepDuration per FaultAnalysisService. |
| PlacementConstraints | stringa, il valore predefinito è ""| Hello PlacementConstraints per FaultAnalysisService. |
| StoredActionCleanupIntervalInSeconds | Int, valore predefinito: 3600 |Questa è la frequenza con cui hello archivio verrà eseguito la pulizia.  Verranno rimosse solo le azioni in stato terminale e completate da un numero di secondi pari almeno a CompletedActionKeepDurationInSeconds. |
| CompletedActionKeepDurationInSeconds | Int, valore predefinito: 604800 | Si tratta approssimativamente il tempo tookeep le azioni che sono in uno stato finale.  Questo dipende inoltre StoredActionCleanupIntervalInSeconds; Poiché toocleanup lavoro hello viene eseguita solo per tale intervallo. 604800 equivale a 7 giorni. |
| StoredChaosEventCleanupIntervalInSeconds | Int, valore predefinito: 3600 |Questa è la frequenza con cui hello archivio verrà controllato per la pulizia. Se il numero di hello di eventi è più 30000; pulizia Hello verrà attivato. |

### <a name="section-name-filestoreservice"></a>Nome della sezione: FileStoreService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| NamingOperationTimeout |Tempo in secondi, il valore predefinito è 60 |Specificare l'intervallo di tempo in secondi. timeout di Hello per eseguire l'operazione di denominazione. |
| QueryOperationTimeout | Tempo in secondi, il valore predefinito è 60 |Specificare l'intervallo di tempo in secondi. timeout di Hello per eseguire l'operazione di query. |
| MaxCopyOperationThreads | Uint, valore predefinito: 0 | numero massimo di Hello file paralleli di tale database secondario è possibile copiare dal database primario. '0' == numero di memorie centrali. |
| MaxFileOperationThreads | Uint, valore predefinito: 100 | numero massimo di Hello di thread paralleli consentiti tooperform FileOperations (copiare o spostare) in hello primario. '0' == numero di memorie centrali. |
| MaxStoreOperations | Uint, valore predefinito: 4096 |numero massimo di Hello parallelo transazione delle operazioni di archiviazione consentita sulla replica primaria. '0' == numero di memorie centrali. |
| MaxRequestProcessingThreads | Uint, valore predefinito: 200 |numero massimo di Hello di thread paralleli consentito primario richieste tooprocess hello. '0' == numero di memorie centrali. |
| MaxSecondaryFileCopyFailureThreshold | Uint, valore predefinito: 25| numero massimo di Hello di tentativi di copia file su hello secondario prima di rinunciare. |
| AnonymousAccessEnabled | Bool, valore predefinito: true |Abilitare o disabilitare l'accesso anonimo toohello che filestoreservice condivisioni. |
| PrimaryAccountType | stringa, il valore predefinito è "" |Hello primario AccountType di hello tooACL principale hello FileStoreService condivide. |
| PrimaryAccountUserName | stringa, il valore predefinito è "" |account principale Hello nome utente di hello tooACL principale hello FileStoreService condivisioni. |
| PrimaryAccountUserPassword | SecureString, valore predefinito: vuoto |password dell'account primario Hello di hello tooACL principale hello FileStoreService condivide. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, valore predefinito: vuoto | segreto di password Hello utilizzato come valore di inizializzazione toogenerated stessa password quando si utilizza l'autenticazione NTLM. |
| PrimaryAccountNTLMX509StoreLocation | stringa, il valore predefinito è "LocalMachine"| percorso dell'archivio del certificato X509 hello Hello utilizzato toogenerate HMAC su hello PrimaryAccountNTLMPasswordSecret quando si utilizza l'autenticazione NTLM. |
| PrimaryAccountNTLMX509StoreName | stringa, il valore predefinito è "MY"| nome dell'archivio del certificato X509 hello Hello utilizzato toogenerate HMAC su hello PrimaryAccountNTLMPasswordSecret quando si utilizza l'autenticazione NTLM. |
| PrimaryAccountNTLMX509Thumbprint | stringa, il valore predefinito è ""|identificazione personale di Hello del certificato X509 hello utilizzato toogenerate HMAC su hello PrimaryAccountNTLMPasswordSecret quando si utilizza l'autenticazione NTLM. |
| SecondaryAccountType | stringa, il valore predefinito è ""| Hello secondario AccountType di hello tooACL principale hello FileStoreService condivide. |
| SecondaryAccountUserName | stringa, il valore predefinito è ""| Hello account secondario di nome utente di hello tooACL principale hello FileStoreService condivisioni. |
| SecondaryAccountUserPassword | SecureString, valore predefinito: vuoto |password dell'account secondario Hello di hello tooACL principale hello FileStoreService condivide.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, valore predefinito: vuoto | segreto di password Hello utilizzato come valore di inizializzazione toogenerated stessa password quando si utilizza l'autenticazione NTLM. |
| SecondaryAccountNTLMX509StoreLocation | stringa, il valore predefinito è "LocalMachine" |percorso dell'archivio del certificato X509 hello Hello utilizzato toogenerate HMAC su hello SecondaryAccountNTLMPasswordSecret quando si utilizza l'autenticazione NTLM. |
| SecondaryAccountNTLMX509StoreName | stringa, il valore predefinito è "MY" |nome dell'archivio del certificato X509 hello Hello utilizzato toogenerate HMAC su hello SecondaryAccountNTLMPasswordSecret quando si utilizza l'autenticazione NTLM. |
| SecondaryAccountNTLMX509Thumbprint | stringa, il valore predefinito è ""| identificazione personale di Hello del certificato X509 hello utilizzato toogenerate HMAC su hello SecondaryAccountNTLMPasswordSecret quando si utilizza l'autenticazione NTLM. |

### <a name="section-name-imagestoreservice"></a>Nome della sezione: ImageStoreService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| Enabled |Bool, valore predefinito: false |flag abilitato per ImageStoreService Hello. |
| TargetReplicaSetSize | Int, valore predefinito: 7 |Hello TargetReplicaSetSize per ImageStoreService. |
| MinReplicaSetSize | Int, valore predefinito: 3 |Hello MinReplicaSetSize per ImageStoreService. |
| ReplicaRestartWaitDuration | Tempo in secondi, valore predefinito: 60,0 * 30 | Specificare l'intervallo di tempo in secondi. Hello ReplicaRestartWaitDuration per ImageStoreService. |
| QuorumLossWaitDuration | Tempo in secondi, valore predefinito: MaxValue | Specificare l'intervallo di tempo in secondi. Hello QuorumLossWaitDuration per ImageStoreService. |
| StandByReplicaKeepDuration | Tempo in secondi, valore predefinito: è 3600.0 * 2 | Specificare l'intervallo di tempo in secondi. Hello StandByReplicaKeepDuration per ImageStoreService. |
| PlacementConstraints | stringa, il valore predefinito è "" | Hello PlacementConstraints per ImageStoreService. |
| ClientUploadTimeout | Tempo in secondi, valore predefinito: 1800 |Specificare l'intervallo di tempo in secondi. Il valore di timeout per il caricamento di primo livello richiesta servizio di archiviazione tooImage. |
| ClientCopyTimeout | Tempo in secondi, valore predefinito: 1800 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per la copia principale richiesta servizio di archiviazione tooImage. |
| ClientDownloadTimeout | Tempo in secondi, valore predefinito: 1800 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per il download di primo livello richiesta servizio di archiviazione tooImage |
| ClientListTimeout | Tempo in secondi, valore predefinito: 600 | Specificare l'intervallo di tempo in secondi. Valore di timeout per l'elenco di primo livello richiesta servizio di archiviazione tooImage. |
| ClientDefaultTimeout | Tempo in secondi, valore predefinito: 180 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per tutte le richieste non non caricare e scaricare (ad esempio, esiste; eliminare) tooImage il servizio di archiviazione. |

### <a name="section-name-imagestoreclient"></a>Nome della sezione: ImageStoreClient
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ClientUploadTimeout |Tempo in secondi, valore predefinito: 1800 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per il caricamento di primo livello richiesta servizio di archiviazione tooImage. |
| ClientCopyTimeout | Tempo in secondi, valore predefinito: 1800 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per la copia principale richiesta servizio di archiviazione tooImage. |
|ClientDownloadTimeout | Tempo in secondi, valore predefinito: 1800 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per il download di primo livello richiesta servizio di archiviazione tooImage. |
|ClientListTimeout | Tempo in secondi, valore predefinito: 600 |Specificare l'intervallo di tempo in secondi. Valore di timeout per l'elenco di primo livello richiesta servizio di archiviazione tooImage. |
|ClientDefaultTimeout | Tempo in secondi, valore predefinito: 180 | Specificare l'intervallo di tempo in secondi. Il valore di timeout per tutte le richieste non non caricare e scaricare (ad esempio, esiste; eliminare) tooImage il servizio di archiviazione. |

### <a name="section-name-tokenvalidationservice"></a>Nome della sezione: TokenValidationService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| Providers |stringa, il valore predefinito è "DSTS" |Elenco separato da virgole tooenable i provider di convalida dei token (provider validi sono: DSTS; AAD). Attualmente è possibile abilitare un singolo provider alla volta. |

### <a name="section-name-upgradeorchestrationservice"></a>Nome della sezione: UpgradeOrchestrationService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, valore predefinito: 0 |Hello TargetReplicaSetSize per UpgradeOrchestrationService. |
| MinReplicaSetSize |Int, valore predefinito: 0 | Hello MinReplicaSetSize per UpgradeOrchestrationService.
| ReplicaRestartWaitDuration | Tempo in secondi, valore predefinito: 60 minuti| Specificare l'intervallo di tempo in secondi. Hello ReplicaRestartWaitDuration per UpgradeOrchestrationService. |
| QuorumLossWaitDuration | Tempo in secondi, valore predefinito: MaxValue | Specificare l'intervallo di tempo in secondi. Hello QuorumLossWaitDuration per UpgradeOrchestrationService. |
| StandByReplicaKeepDuration | Tempo in secondi, valore predefinito: 60*24*7 minuti | Specificare l'intervallo di tempo in secondi. Hello StandByReplicaKeepDuration per UpgradeOrchestrationService. |
| PlacementConstraints | stringa, il valore predefinito è "" | Hello PlacementConstraints per UpgradeOrchestrationService. |
| AutoupgradeEnabled | Bool, valore predefinito: true | Polling e aggiornamenti automatici in base a un file di stato obiettivo. |
| UpgradeApprovalRequired | Bool, valore predefinito: false | Aggiornamento del codice di impostazione toomake richiedono l'approvazione dell'amministratore prima di procedere. |

### <a name="section-name-upgradeservice"></a>Nome della sezione: UpgradeService
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| PlacementConstraints |stringa, il valore predefinito è "" |Hello PlacementConstraints per il servizio di aggiornamento. |
| TargetReplicaSetSize | Int, valore predefinito: 3 | Hello TargetReplicaSetSize per UpgradeService. |
| MinReplicaSetSize | Int, valore predefinito: 2 | Hello MinReplicaSetSize per UpgradeService. |
| CoordinatorType | stringa, il valore predefinito è "WUTest"| Hello CoordinatorType per UpgradeService. |
| BaseUrl | stringa, il valore predefinito è "" |BaseUrl per UpgradeService. |
| ClusterId | stringa, il valore predefinito è "" | ClusterId per UpgradeService. |
| X509StoreName | stringa, il valore predefinito è "My"| X509StoreName per UpgradeService. |
| X509StoreLocation | stringa, il valore predefinito è "" | X509StoreLocation per UpgradeService. |
| X509FindType | stringa, il valore predefinito è ""| X509FindType per UpgradeService. |
| X509FindValue | stringa, il valore predefinito è "" | X509FindValue per UpgradeService. |
| X509SecondaryFindValue | stringa, il valore predefinito è "" | X509SecondaryFindValue per UpgradeService. |
| OnlyBaseUpgrade | Bool, valore predefinito: false | OnlyBaseUpgrade per UpgradeService. |
| TestCabFolder | stringa, il valore predefinito è "" | TestCabFolder per UpgradeService. |

### <a name="section-name-securityclientaccess"></a>Nome della sezione: Security/ClientAccess
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| CreateName |stringa, il valore predefinito è "Admin" |Configurazione di sicurezza per creare un URI di denominazione. |
| DeleteName |stringa, il valore predefinito è "Admin" |Configurazione di sicurezza per eliminare un URI di denominazione. |
| PropertyWriteBatch |stringa, il valore predefinito è "Admin" |Configurazione di sicurezza per le operazioni di scrittura di proprietà di denominazione. |
| CreateService |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per creare un servizio. |
| CreateServiceFromTemplate |stringa, il valore predefinito è "Admin" |Configurazione di sicurezza per creare un servizio da un modello. |
| UpdateService |stringa, il valore predefinito è "Admin" |Configurazione di sicurezza per gli aggiornamenti dei servizi. |
| DeleteService  |stringa, il valore predefinito è "Admin" |Configurazione di sicurezza per eliminare un servizio. |
| ProvisionApplicationType |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per il provisioning dei tipi di applicazione. |
| CreateApplication |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per creare un'applicazione. |
| DeleteApplication |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per eliminare un'applicazione. |
| UpgradeApplication |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per avviare o interrompere gli aggiornamenti dell'applicazione. |
| RollbackApplicationUpgrade |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per eseguire il rollback degli aggiornamenti dell'applicazione. |
| UnprovisionApplicationType |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per annullare il provisioning dei tipi di applicazione. |
| MoveNextUpgradeDomain |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per riprendere gli aggiornamenti dell'applicazione con un dominio di aggiornamento esplicito. |
| ReportUpgradeHealth |stringa, il valore predefinito è "Admin" | Configurazione della sicurezza per gli aggiornamenti dell'applicazione con lo stato dell'aggiornamento corrente hello ripresa. |
| ReportHealth |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per i report di integrità. |
| ProvisionFabric |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per il provisioning del manifesto del cluster e/o del file con estensione msi. |
| UpgradeFabric |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per avviare gli aggiornamenti del cluster. |
| RollbackFabricUpgrade |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per il rollback degli aggiornamenti del cluster. |
| UnprovisionFabric |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per l'annullamento del provisioning del manifesto del cluster e/o del file con estensione msi. |
| MoveNextFabricUpgradeDomain |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per riprendere gli aggiornamenti del cluster con un dominio di aggiornamento esplicito. |
| ReportFabricUpgradeHealth |stringa, il valore predefinito è "Admin" | Configurazione della sicurezza per gli aggiornamenti di cluster con lo stato dell'aggiornamento corrente hello ripresa. |
| StartInfrastructureTask |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per avviare le attività di infrastruttura. |
| FinishInfrastructureTask |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per terminare le attività di infrastruttura. |
| ActivateNode |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per attivare un nodo. |
| DeactivateNode |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per disattivare un nodo. |
| DeactivateNodesBatch |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per disattivare più nodi. |
| RemoveNodeDeactivations |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per annullare la disattivazione di più nodi. |
| GetNodeDeactivationStatus |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per controllare lo stato di disattivazione. |
| NodeStateRemoved |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per i report sulla rimozione dello stato di un nodo. |
| RecoverPartition |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per ripristinare una partizione. |
| RecoverPartitions |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per ripristinare più partizioni. |
| RecoverServicePartitions |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per ripristinare partizioni di servizio. |
| RecoverSystemPartitions |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per ripristinare partizioni di servizio di sistema. |
| ReportFault |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per i report di errori. |
| InvokeInfrastructureCommand |stringa, il valore predefinito è "Admin" | Configurazione di protezione per i comandi di gestione delle attività di infrastruttura. |
| FileContent |stringa, il valore predefinito è "Admin" | Configurazione della sicurezza per l'immagine di archiviare il trasferimento di file client (toocluster esterno). |
| FileDownload |stringa, il valore predefinito è "Admin" | Configurazione della sicurezza per image store client file download avvio (toocluster esterno). |
| InternalList |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per l'operazione di elenco del file del client dell'archivio immagini (interno). |
| Elimina |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per l'operazione di eliminazione del client dell'archivio immagini. |
| Carica |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per l'operazione di copia del client dell'archivio immagini. |
| GetStagingLocation |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per il recupero del percorso di gestione temporanea del client dell'archivio immagini. |
| GetStoreLocation |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per il recupero del percorso dell'archivio del client dell'archivio immagini. |
| NodeControl |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per avviare, arrestare e riavviare i nodi. |
| CodePackageControl |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per riavviare i pacchetti di codice. |
| UnreliableTransportControl |stringa, il valore predefinito è "Admin" | Trasporto non affidabile per l'aggiunta e la rimozione di comportamenti. |
| MoveReplicaControl |stringa, il valore predefinito è "Admin" | Spostamento di repliche. |
| PredeployPackageToNode |stringa, il valore predefinito è "Admin" | API per la pre-distribuzione. |
| StartPartitionDataLoss |stringa, il valore predefinito è "Admin" | Provoca la perdita di dati in una partizione. |
| StartPartitionQuorumLoss |stringa, il valore predefinito è "Admin" | Provoca la perdita di quorum in una partizione. |
| StartPartitionRestart |stringa, il valore predefinito è "Admin" | Riavvia contemporaneamente alcune o tutte le repliche di hello di una partizione. |
| CancelTestCommand |stringa, il valore predefinito è "Admin" | Annulla un TestCommand specifico, se è in corso. |
| StartChaos |stringa, il valore predefinito è "Admin" | Avvia Chaos, se non è già avviato. |
| StopChaos |stringa, il valore predefinito è "Admin" | Arresta Chaos, se è stato avviato. |
| StartNodeTransition |stringa, il valore predefinito è "Admin" | Configurazione di sicurezza per avviare la transizione di un nodo. |
| StartClusterConfigurationUpgrade |stringa, il valore predefinito è "Admin" | Provoca StartClusterConfigurationUpgrade in una partizione. |
| GetUpgradesPendingApproval |stringa, il valore predefinito è "Admin" | Provoca GetUpgradesPendingApproval in una partizione. |
| StartApprovedUpgrades |stringa, il valore predefinito è "Admin" | Provoca StartApprovedUpgrades in una partizione. |
| Ping |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per i ping di client. |
| Query |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per le query. |
| NameExists |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per i controlli sulla presenza di URI di denominazione. |
| EnumerateSubnames |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per l'enumerazione degli URI di denominazione. |
| EnumerateProperties |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per l'enumerazione delle proprietà di denominazione. |
| PropertyReadBatch |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per le operazioni di lettura delle proprietà di denominazione. |
| GetServiceDescription |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per le notifiche del servizio di long polling e lettura delle descrizioni dei servizi. |
| ResolveService |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per la risoluzione di servizi in base a reclami. |
| ResolveNameOwner |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per la risoluzione dei proprietari degli URI di denominazione. |
| ResolvePartition |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per la risoluzione dei servizi di sistema. |
| ServiceNotifications |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per le notifiche di servizi basati su eventi. |
| PrefixResolveService |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per la risoluzione dei prefissi di basati sui reclami. |
| GetUpgradeStatus |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per il polling dello stato degli aggiornamenti dell'applicazione. |
| GetFabricUpgradeStatus |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per il polling dello stato degli aggiornamenti del cluster. |
| InvokeInfrastructureQuery |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per eseguire query sulle attività di infrastruttura. |
| Elenco |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per l'operazione di elenco del file del client dell'archivio immagini. |
| ResetPartitionLoad |stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per reimpostare il carico per failoverUnit. |
| ToggleVerboseServicePlacementHealthReporting | stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per attivare o disattivare ServicePlacement HealthReporting dettagliati. |
| GetPartitionDataLossProgress | stringa, il valore predefinito è "Admin\|\|User" | Recupera lo stato di avanzamento hello per una chiamata di api invoke perdita dati. |
| GetPartitionQuorumLossProgress | stringa, il valore predefinito è "Admin\|\|User" | Recupera lo stato di avanzamento hello per una chiamata di api perdita di quorum invoke. |
| GetPartitionRestartProgress | stringa, il valore predefinito è "Admin\|\|User" | Recupera lo stato di avanzamento hello per una chiamata all'api di riavvio partizione. |
| GetChaosReport | stringa, il valore predefinito è "Admin\|\|User" | Recupera lo stato di hello di Chaos entro un intervallo di tempo specificato. |
| GetNodeTransitionProgress | stringa, il valore predefinito è "Admin\|\|User" | Configurazione di sicurezza per recuperare lo stato di avanzamento di un comando di transizione nodo. |
| GetClusterConfigurationUpgradeStatus | stringa, il valore predefinito è "Admin\|\|User" | Provoca GetClusterConfigurationUpgradeStatus in una partizione. |
| GetClusterConfiguration | stringa, il valore predefinito è "Admin\|\|User" | Provoca GetClusterConfiguration in una partizione. |

### <a name="section-name-reconfigurationagent"></a>Nome della sezione: ReconfigurationAgent
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Tempo in secondi, valore predefinito: 900 |Specificare l'intervallo di tempo in secondi. durata Hello per i quali hello sistema attenderà prima di interrompere gli host del servizio che dispongono di repliche che sono bloccate in chiusura. |
| ServiceApiHealthDuration | Tempo in secondi, valore predefinito: 30 minuti | Specificare l'intervallo di tempo in secondi. ServiceApiHealthDuration definisce quanto tempo si si resta in attesa per un toorun API servizio prima di un report è il tipo non integro. |
| ServiceReconfigurationApiHealthDuration | Tempo in secondi, il valore predefinito è 30 | Specificare l'intervallo di tempo in secondi. ServiceReconfigurationApiHealthDuration definisce quanto tempo hello prima di un servizio in riconfigurazione è segnalato come non integro. |
| PeriodicApiSlowTraceInterval | Tempo in secondi, valore predefinito: 5 minuti | Specificare l'intervallo di tempo in secondi. PeriodicApiSlowTraceInterval definisce l'intervallo di hello su cui è verranno ridisegnate chiamate API lente dal monitoraggio API hello. |
| NodeDeactivationMaxReplicaCloseDuration | Tempo in secondi, valore predefinito: 900 | Specificare l'intervallo di tempo in secondi. Hello toowait tempo massimo prima della chiusura di un host del servizio che sta bloccando la disattivazione del nodo. |
| FabricUpgradeMaxReplicaCloseDuration | Tempo in secondi, valore predefinito: 900 | Specificare l'intervallo di tempo in secondi. Hello durata massima RA attenderà prima di interrompere l'host del servizio di replica che non viene chiusa. |
| IsDeactivationInfoEnabled | Bool, valore predefinito: true | Determina se RA utilizzerà le informazioni di disattivazione per l'esecuzione di elezione nuovamente primario per i cluster di nuovo questa configurazione deve essere impostata tootrue per i cluster esistenti vengono aggiornati, vedere le note sulla versione di hello sul tooenable questo. |

### <a name="section-name-placementandloadbalancing"></a>Nome della sezione: PlacementAndLoadBalancing
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| TraceCRMReasons |Bool, valore predefinito: true |Specifica se canale gli eventi operativi di spostamenti di tipo toohello tootrace motivi per CRM. |
| ValidatePlacementConstraint | Bool, valore predefinito: true | Specifica se consentire o meno hello PlacementConstraint espressione per un servizio viene convalidato quando viene aggiornata ServiceDescription di un servizio. |
| PlacementConstraintValidationCacheSize | Int, valore predefinito: 10000 | Limiti hello dimensioni della tabella hello utilizzato per la convalida rapida e la memorizzazione nella cache la selezione host delle espressioni di vincolo. |
|VerboseHealthReportLimit | Int, valore predefinito: 20 | Definisce hello numero di volte in cui che una replica ha non spostato toogo prima di un avviso di integrità viene segnalato per tale (se è abilitata segnalazione dettagliata integrità). |
|ConstraintViolationHealthReportLimit | Int, valore predefinito: 50 | Definisce hello numero di volte in cui il vincolo violano replica dispone di toobe unfixed in modo permanente prima di diagnostica viene effettuata e vengono generati rapporti di stato. |
|DetailedConstraintViolationHealthReportLimit | Int, valore predefinito: 200 | Definisce hello numero di volte in cui il vincolo violano replica dispone di toobe unfixed in modo permanente prima di diagnostica viene effettuata e vengono generati i report di stato dettagliate. |
|DetailedVerboseHealthReportLimit | Int, valore predefinito: 200 | Definisce il numero di hello di volte in cui che una replica unplaced deve toobe unplaced in modo permanente prima di stato dettagliate vengono generati i report. |
|ConsecutiveDroppedMovementsHealthReportLimit | Int, valore predefinito: 20 | Definisce il numero di hello di volte consecutive che rilasciato ResourceBalancer spostamenti di tipo vengono eliminati prima di diagnostica viene effettuata e vengono generati avvisi di integrità. Valore negativo: non vengono emessi avvisi. |
|DetailedNodeListLimit | Int, valore predefinito: 15 | Definisce il numero di hello di nodi per tooinclude vincolo prima di troncamento in hello che replica non spostati i report. |
|DetailedPartitionListLimit | Int, valore predefinito: 15 | Definisce il numero di hello di partizioni per ogni voce di diagnostica per un vincolo di tooinclude prima di troncamento nella diagnostica. |
|DetailedDiagnosticsInfoListLimit | Int, valore predefinito: 15 | Definisce il numero di hello di voci di diagnostiche (con informazioni dettagliate) per ogni vincolo tooinclude prima il troncamento in diagnostica.|
|PLBRefreshGap | Tempo in secondi, valore predefinito: 1 | Specificare l'intervallo di tempo in secondi. Definisce hello quantità minima di tempo che deve trascorrere prima PLB Aggiorna stato nuovo. |
|MinPlacementInterval | Tempo in secondi, valore predefinito: 1 | Specificare l'intervallo di tempo in secondi. Definisce una quantità minima di hello di tempo che deve trascorrere prima di due cicli consecutivi di posizionamento. |
|MinConstraintCheckInterval | Tempo in secondi, valore predefinito: 1 | Specificare l'intervallo di tempo in secondi. Definisce una quantità minima di hello di tempo che deve trascorrere prima di vincolo consecutivi due cicli di archiviazione. |
|MinLoadBalancingInterval | Tempo in secondi, valore predefinito: 5 | Specificare l'intervallo di tempo in secondi. Definisce una quantità minima di hello di tempo che deve trascorrere prima di due cicli di bilanciamento del carico consecutivi. |
|BalancingDelayAfterNodeDown | Tempo in secondi, valore predefinito: 120 |Specificare l'intervallo di tempo in secondi. Non avviare attività di bilanciamento in questo periodo se un nodo va offline. |
|BalancingDelayAfterNewNode | Tempo in secondi, valore predefinito: 120 |Specificare l'intervallo di tempo in secondi. Non avviare attività di bilanciamento in questo periodo dopo aver aggiunto un nuovo nodo. |
|ConstraintFixPartialDelayAfterNodeDown | Tempo in secondi, valore predefinito: 120 | Specificare l'intervallo di tempo in secondi. Non risolvere violazioni di vincoli FaultDomain e UpgradeDomain in questo periodo dopo che un nodo va offline. |
|ConstraintFixPartialDelayAfterNewNode | Tempo in secondi, valore predefinito: 120 | Specificare l'intervallo di tempo in secondi. Non risolvere violazioni di vincoli FaultDomain e UpgradeDomain in questo periodo dopo aver aggiunto un nuovo nodo. |
|GlobalMovementThrottleThreshold | Uint, valore predefinito: 1000 | Numero massimo di spostamenti di tipo consentito in hello fase bilanciamento del carico in hello precedente intervallo indicato da GlobalMovementThrottleCountingInterval. |
|GlobalMovementThrottleThresholdForPlacement | Uint, valore predefinito: 0 | Numero massimo di spostamenti di tipo consentito nella fase di selezione host hello precedente intervallo indicato da GlobalMovementThrottleCountingInterval.0 indica nessun limite.|
|GlobalMovementThrottleThresholdForBalancing | Uint, valore predefinito: 0 | Numero massimo di spostamenti di tipo consentito nella fase di bilanciamento del carico hello precedente intervallo indicato da GlobalMovementThrottleCountingInterval. Impostarlo su 0 per non avere limiti. |
|GlobalMovementThrottleCountingInterval | Tempo in secondi, valore predefinito: 600 | Specificare l'intervallo di tempo in secondi. Indicare la lunghezza hello di hello oltre l'intervallo per cui tootrack per i movimenti di replica dominio (usato insieme a GlobalMovementThrottleThreshold). È possibile impostare too0 tooignore limitazione completamente globali. |
|MovementPerPartitionThrottleThreshold | Uint, valore predefinito: 50 | Nessun bilanciamento del correlate movimento verificherà per una partizione se numero hello di bilanciamento del carico spostamenti correlati per le repliche di tale partizione ha raggiunto o superato MovementPerFailoverUnitThrottleThreshold in hello ultimi intervallo indicato da MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Tempo in secondi, valore predefinito: 600 | Specificare l'intervallo di tempo in secondi. Indicare la lunghezza hello di hello oltre l'intervallo per i quali replica tootrack movimenti per ogni partizione (usato insieme a MovementPerPartitionThrottleThreshold). |
|PlacementSearchTimeout | Tempo in secondi, valore predefinito: 0.5 | Specificare l'intervallo di tempo in secondi. Tempo massimo di ricerca durante il posizionamento dei servizi prima di restituire un risultato. |
|UseMoveCostReports | Bool, valore predefinito: false | Indica l'elemento hello LB tooignore hello costo di hello assegnazione dei punteggi di funzione. numero potenzialmente elevato risulta degli spostamenti per migliorare la selezione bilanciato. |
|PreventTransientOvercommit | Bool, valore predefinito: false | Determina deve PLB immediatamente contare sulle risorse che verranno liberate da passa hello avviata. Per impostazione predefinita. PLB può avviare spostamento out e spostare hello stesso nodo che è possibile creare temporaneo overcommit. Impostazione tootrue questo parametro sarà in grado di quelli di overcommits e deframmentazione su richiesta (noto anche come placementWithMove) verrà disabilitata. |
|InBuildThrottlingEnabled | Bool, valore predefinito: false | Determinare se è abilitata la limitazione delle richieste di hello nella compilazione. |
|InBuildThrottlingAssociatedMetric | stringa, il valore predefinito è "" | Hello è associato il nome della metrica per questa limitazione. |
|InBuildThrottlingGlobalMaxValue | Int, valore predefinito: 0 |numero massimo di Hello di repliche nella compilazione consentito a livello globale. |
|SwapPrimaryThrottlingEnabled | Bool, valore predefinito: false| Determinare se è abilitata la limitazione delle richieste di hello swap primario. |
|SwapPrimaryThrottlingAssociatedMetric | stringa, il valore predefinito è ""| Hello è associato il nome della metrica per questa limitazione. |
|SwapPrimaryThrottlingGlobalMaxValue | Int, valore predefinito: 0 | numero massimo di Hello di repliche di scambio primario consentito a livello globale. |
|PlacementConstraintPriority | Int, valore predefinito: 0 | Determina la priorità di hello del vincolo di posizionamento: 0: rigido; 1: software; negativo: ignorare. |
|PreferredLocationConstraintPriority | Int, valore predefinito: 2| Determina la priorità di hello del vincolo di percorso preferito: 0: rigido; 1: software; 2: ottimizzazione; negativo: ignorare |
|CapacityConstraintPriority | Int, valore predefinito: 0 | Determina la priorità di hello del vincolo di capacità: 0: rigido; 1: software; negativo: ignorare. |
|AffinityConstraintPriority | Int, valore predefinito: 0 | Determina la priorità di hello del vincolo di affinità: 0: rigido; 1: software; negativo: ignorare. |
|FaultDomainConstraintPriority | Int, valore predefinito: 0 | Determina la priorità di hello del vincolo di dominio di errore: 0: rigido; 1: software; negativo: ignorare. |
|UpgradeDomainConstraintPriority | Int, valore predefinito: 1| Determina la priorità di hello del vincolo di dominio di aggiornamento: 0: rigido; 1: software; negativo: ignorare. |
|ScaleoutCountConstraintPriority | Int, valore predefinito: 0 | Determina la priorità di hello del vincolo di conteggio di scalabilità orizzontale: 0: rigido; 1: software; negativo: ignorare. |
|ApplicationCapacityConstraintPriority | Int, valore predefinito: 0 | Determina la priorità di hello del vincolo di capacità: 0: rigido; 1: software; negativo: ignorare. |
|MoveParentToFixAffinityViolation | Bool, valore predefinito: false | L'impostazione che determina se le repliche padre possono essere spostati toofix vincoli di affinità.|
|MoveExistingReplicaForPlacement | Bool, valore predefinito: true |Impostazione che determina se toomove replica esistente durante la selezione host. |
|UseSeparateSecondaryLoad | Bool, valore predefinito: true | Impostazione che determina se usare un carico secondario differente. |
|PlaceChildWithoutParent | Bool, valore predefinito: true | Impostazione che determina se è possibile posizionare una replica di servizio figlia in caso non sia presente una replica padre. |
|PartiallyPlaceServices | Bool, valore predefinito: true | Determina se tutte le repliche servizio nel cluster verranno posizionate in modo "tutto o niente" in caso di nodi appropriati limitati.|
|InterruptBalancingForAllFailoverUnitUpdates | Bool, valore predefinito: false | Determina se qualsiasi tipo di aggiornamento di un'unità di failover deve interrompere un'esecuzione di un bilanciamento rapido o lento. Specificare "false" per interrompere l'esecuzione del bilanciamento se FailoverUnit: viene creata/eliminata; ha repliche mancanti; ha modificato il percorso di replica primario o il numero di repliche. L'esecuzione del bilanciamento NON verrà interrotta in altri casi, ossia se FailoverUnit: ha repliche extra; ha modificato flag della replica; ha modificato solo la versione della partizione e tutti gli altri casi. |

### <a name="section-name-security"></a>Nome della sezione: Security
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ClusterProtectionLevel |Nessuno o EncryptAndSign |Nessuno (predefinito) per i cluster non protetti, EncryptAndSign per i cluster protetti. |

### <a name="section-name-hosting"></a>Nome della sezione: Hosting
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Tempo in secondi, il valore predefinito è 300 |Tempo massimo consentito per hello ServiceType toobe registrato con l'infrastruttura |
| ServiceTypeDisableFailureThreshold |Numero intero, il valore predefinito è 1 |Si tratta di soglia di hello per il conteggio degli errori dopo la quale è FailoverManager (FM) hello notificato toodisable il tipo di servizio di hello in tale nodo e provare a un nodo diverso per la selezione host. |
| ActivationRetryBackoffInterval |Tempo in secondi, il valore predefinito è 5 |Intervallo di Backoff in ogni caso di errore di attivazione; In ogni caso di errore di attivazione continua, i tentativi di sistema hello hello attivazione per backup toohello MaxActivationFailureCount. intervallo tra tentativi Hello ogni tentativo è un prodotto di attivazione continua errore e hello Backoff intervallo di attivazione. |
| ActivationMaxRetryInterval |Tempo in secondi, il valore predefinito è 300 |In ogni caso di errore di attivazione continua, i tentativi di sistema hello hello attivazione per backup tooActivationMaxFailureCount. ActivationMaxRetryInterval specifica l'intervallo di tempo di attesa prima di un nuovo tentativo dopo ogni errore di attivazione |
| ActivationMaxFailureCount |Numero intero, il valore predefinito è 10 |Numero di volte che il sistema ritenta l'attivazione non riuscita prima di rinunciare |

### <a name="section-name-failovermanager"></a>Nome della sezione: FailoverManager
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Tempo in secondi, il valore predefinito è 10 |Determina la frequenza con cui hello controllo FM per i nuovi report di carico |

### <a name="section-name-federation"></a>Nome della sezione: Federation
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| LeaseDuration |Tempo in secondi, il valore predefinito è 30 |Durata di un lease tra un nodo e gli elementi adiacenti. |
| LeaseDurationAcrossFaultDomain |Tempo in secondi, il valore predefinito è 30 |Durata di un lease tra un nodo e gli elementi adiacenti nei domini di errore. |

### <a name="section-name-clustermanager"></a>Nome della sezione: ClusterManager
| **Parametro** | **Valori consentiti** | **Indicazioni o breve descrizione** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Tempo in secondi, il valore predefinito è 60 |frequenza di Hello del polling per stato di aggiornamento dell'applicazione. Questo valore determina la frequenza hello dell'aggiornamento per qualsiasi chiamata GetApplicationUpgradeProgress |
| UpgradeHealthCheckInterval |Tempo in secondi, il valore predefinito è 60 |Controlla la frequenza di Hello dello stato di integrità durante un aggiornamento dell'applicazione monitorata |
| FabricUpgradeStatusPollInterval |Tempo in secondi, il valore predefinito è 60 |frequenza di Hello del polling per stato di aggiornamento dell'infrastruttura. Questo valore determina la frequenza hello dell'aggiornamento per qualsiasi chiamata GetFabricUpgradeProgress |
| FabricUpgradeHealthCheckInterval |Tempo in secondi, il valore predefinito è 60 |frequenza di Hello del controllo di stato di integrità durante un aggiornamento dell'infrastruttura monitorato |
|InfrastructureTaskProcessingInterval | Tempo in secondi, il valore predefinito è 10 |Specificare l'intervallo di tempo in secondi. intervallo di elaborazione Hello utilizzato dal computer di stato di elaborazione delle attività dell'infrastruttura hello. |
|TargetReplicaSetSize |Int, valore predefinito: 7 |Hello TargetReplicaSetSize per ClusterManager. |
|MinReplicaSetSize |Int, valore predefinito: 3 |Hello MinReplicaSetSize per ClusterManager. |
|ReplicaRestartWaitDuration |Tempo in secondi, valore predefinito: (60.0 * 30)|Specificare l'intervallo di tempo in secondi. Hello ReplicaRestartWaitDuration per ClusterManager. |
|QuorumLossWaitDuration |Tempo in secondi, valore predefinito: MaxValue | Specificare l'intervallo di tempo in secondi. Hello QuorumLossWaitDuration per ClusterManager. |
|StandByReplicaKeepDuration | Tempo in secondi, valore predefinito: (3600.0 * 2)|Specificare l'intervallo di tempo in secondi. Hello StandByReplicaKeepDuration per ClusterManager. |
|PlacementConstraints | stringa, il valore predefinito è "" |Hello PlacementConstraints per ClusterManager. |
|SkipRollbackUpdateDefaultService | Bool, valore predefinito: false |Hello CM ignorerà i servizi di ripristino predefinito aggiornato durante il rollback dell'aggiornamento dell'applicazione. |
|EnableDefaultServicesUpgrade | Bool, valore predefinito: false |Abilita l'aggiornamento dei servizi predefiniti durante l'aggiornamento dell'applicazione. Le descrizioni dei servizi predefiniti vengono sovrascritte in seguito all'aggiornamento. |
|InfrastructureTaskHealthCheckWaitDuration |Tempo in secondi, valore predefinito: 0| Specificare l'intervallo di tempo in secondi. quantità di Hello di toowait tempo prima di avviare i controlli di integrità dopo un'operazione dell'infrastruttura di post-elaborazione. |
|InfrastructureTaskHealthCheckStableDuration | Tempo in secondi, valore predefinito: 0| Specificare l'intervallo di tempo in secondi. quantità di Hello di tempo tooobserve passato dell'integrità consecutivi controlla prima di post-elaborazione di un'attività dell'infrastruttura viene completata correttamente. In caso di un controllo di integrità negativo, il timer verrà reimpostato. |
|InfrastructureTaskHealthCheckRetryTimeout | Tempo in secondi, il valore predefinito è 60 |Specificare l'intervallo di tempo in secondi. quantità di Hello di tempo toospend nuovo tentativo in corso controlli di integrità non riuscita durante un'operazione dell'infrastruttura di post-elaborazione. In caso di un controllo di integrità positivo, il timer verrà reimpostato. |
|ImageBuilderTimeoutBuffer |Tempo in secondi, valore predefinito: 3 |Specificare l'intervallo di tempo in secondi. quantità di Hello di tooallow ora per il client di Image Builder timeout specifico errori tooreturn toohello. Se il buffer è troppo piccolo. quindi client hello scade prima che il server di hello e ottiene un errore di timeout generico. |
|MinOperationTimeout | Tempo in secondi, il valore predefinito è 60 |Specificare l'intervallo di tempo in secondi. Hello globale timeout minimo per l'elaborazione delle operazioni su ClusterManager internamente. |
|MaxOperationTimeout |Tempo in secondi, valore predefinito: MaxValue | Specificare l'intervallo di tempo in secondi. Hello globale timeout massimo per l'elaborazione delle operazioni su ClusterManager internamente. |
|MaxTimeoutRetryBuffer | Tempo in secondi, valore predefinito: 600 |Specificare l'intervallo di tempo in secondi. timeout dell'operazione massimo Hello quando internamente nuovo tentativo di scadenza è tootimeouts <Original Timeout>  +  <MaxTimeoutRetryBuffer>. Viene aggiunto timeout aggiuntivo in incrementi di MinOperationTimeout. |
|MaxCommunicationTimeout |Tempo in secondi, valore predefinito: 600 |Specificare l'intervallo di tempo in secondi. Hello timeout massimo per le comunicazioni interne tra ClusterManager e altri servizi di sistema (ad esempio; Servizio di denominazione. Failover Manager e così via). Questo timeout deve essere inferiore a MaxOperationTimeout globale, poiché potrebbero avvenire più comunicazioni tra i componenti di sistema per ciascuna operazione client. |
|MaxDataMigrationTimeout |Tempo in secondi, valore predefinito: 600 |Specificare l'intervallo di tempo in secondi. Dopo un aggiornamento di Fabric ha avuto luogo, Hello timeout massimo per le operazioni di ripristino di dati della migrazione. |
|MaxOperationRetryDelay |Tempo in secondi, valore predefinito: 5| Specificare l'intervallo di tempo in secondi. ritardo massimo di Hello per i tentativi interni quando vengono rilevati errori. |
|ReplicaSetCheckTimeoutRollbackOverride |Tempo in secondi, valore predefinito: 1200 | Specificare l'intervallo di tempo in secondi. Se ReplicaSetCheckTimeout è impostato un valore massimo di toohello DWORD; quindi ne viene eseguito l'override con valore hello di questa configurazione per scopi di hello del rollback. valore Hello utilizzato per il rollforward non viene mai eseguito l'override. |
|ImageBuilderJobQueueThrottle |Int, valore predefinito: 10 |Limitazione del conteggio dei thread per le code di processi di Image Builder nelle richieste di applicazione. |

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla gestione del cluster, leggere questi articoli:

[Aggiunta, rollover e rimozione di certificati dal cluster di Azure ](service-fabric-cluster-security-update-certs-azure.md) 

