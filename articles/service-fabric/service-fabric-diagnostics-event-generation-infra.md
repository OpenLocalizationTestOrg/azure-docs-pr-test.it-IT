---
title: Monitoraggio livello di servizio dell'infrastruttura della piattaforma aaaAzure | Documenti Microsoft
description: Informazioni su eventi a livello di piattaforma e log utilizzato toomonitor e diagnosticare i cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Generazione di eventi e log a livello piattaforma

## <a name="monitoring-hello-cluster"></a>Monitoraggio cluster hello

È importante toomonitor al livello toodetermine piattaforma hello o meno l'hardware e il cluster si comportino nel modo previsto. Anche se Service Fabric è possibile mantenere le applicazioni in esecuzione durante un errore hardware, ma è comunque necessario toodiagnose se si verifica un errore in un'applicazione o nell'infrastruttura sottostante hello. È anche necessario monitorare il piano toobetter cluster per la capacità, contribuendo nelle decisioni sull'aggiunta o rimozione di hardware.

Service Fabric fornisce cinque log diverso canali out-of-the-box che generano hello seguenti eventi:

* Canale operativo: operazioni di alto livello dell'infrastruttura di servizio e cluster hello, inclusi gli eventi per un nodo a presentarsi, una nuova applicazione distribuita, o un SF aggiornare rollback e così via.
* Canale di informazioni operativo: report di integrità e decisioni di bilanciamento del carico
* Canale messaggistica & dati: log critici e gli eventi generati messaggistica (attualmente solo hello ReverseProxy) e il percorso dei dati (modelli di servizi affidabili)
* Canale messaggistica & dati - dettagliate: canale dettagliato che contiene tutti i registri non critici hello dai dati e di messaggistica in cluster hello (questo canale è un volume molto elevato di eventi)   
* [Eventi di Reliable Services](service-fabric-reliable-services-diagnostics.md): eventi specifici del modello di programmazione
* [Eventi di Reliable Actors](service-fabric-reliable-actors-diagnostics.md): eventi e contatori delle prestazioni specifici del modello di programmazione
* Supporta i log: i registri di sistema generati da toobe solo di Service Fabric utilizzato da Microsoft, quando viene fornito supporto

Questi vari canali coprono la maggior parte delle hello piattaforma registrazione a livello di cui è consigliata. livello piattaforma tooimprove registrazione, è consigliabile investire in una migliore comprensione hello modello di integrità e aggiungere i rapporti di stato personalizzati e aggiunta personalizzato **i contatori delle prestazioni** toobuild una conoscenza di hello in tempo reale impatto di i servizi e applicazioni in cluster hello.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Creazione di report su integrità e carico di Azure Service Fabric

Service Fabric offre un modello di integrità specifico, descritto in dettaglio in questi articoli:
- [Il monitoraggio dello stato dell'infrastruttura di introduzione tooService](service-fabric-health-introduction.md)
- [Creare report e verificare l'integrità dei servizi](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Aggiungere report sull'integrità di Service Fabric personalizzati](service-fabric-report-health.md)
- [Come visualizzare i report sull'integrità di Service Fabric](service-fabric-view-entities-aggregated-health.md)

Il monitoraggio dello stato è critico toomultiple aspetti dell'esecuzione di un servizio. Il monitoraggio dell'integrità è particolarmente importante quando Service Fabric esegue l'aggiornamento di un'applicazione denominata. Dopo ogni dominio di aggiornamento del servizio hello è aggiornata e non è disponibile tooyour clienti, dominio di aggiornamento hello deve superare controlli di integrità prima distribuzione hello Sposta toohello dominio di aggiornamento successivo. Se non è possibile ottenere lo stato di integrità buono, distribuzione hello viene eseguito il rollback, in modo che un'applicazione hello è in uno stato valido noto. Anche se alcuni clienti possono essere influenzati prima di eseguire il rollback servizi hello, la maggior parte dei clienti non riscontrare un problema. Una risoluzione viene eseguita anche relativamente rapidamente e senza toowait per l'azione da un operatore umano. Hello ulteriori controlli di integrità che sono incorporati nel codice, hello più flessibile, che il servizio è toodeployment problemi.

Le metriche dal servizio hello segnala un altro aspetto dell'integrità del servizio. Le metriche sono importanti nell'infrastruttura del servizio poiché si tratta dell'utilizzo delle risorse toobalance utilizzato. Possono anche essere usate come un indicatore dell'integrità del sistema. È ad esempio possibile che sia presente un'applicazione con molti servizi e che ogni istanza segnali una metrica relativa alle richieste al secondo. Se un servizio utilizza più risorse rispetto a un altro servizio, Service Fabric sposta le istanze del servizio cluster hello, l'utilizzo delle risorse anche toomaintain tootry. Per una spiegazione più dettagliata del funzionamento dell'utilizzo delle risorse, vedere [Gestione dell'utilizzo delle risorse e del carico in Service Fabric con le metriche](service-fabric-cluster-resource-manager-metrics.md).

Le metriche consentono anche di ottenere informazioni approfondite sulle prestazioni del servizio. Nel corso del tempo, è possibile utilizzare toocheck metriche che servizio hello sta operando all'interno di parametri previsti. Se, ad esempio, le tendenze mostrano che alle 9.00 su hello lunedì mattina medio RPS è 1.000, quindi è possibile impostare un rapporto di stato che genera avvisi se hello RPS è inferiore a 500 o superiore 1.500. Tutto ciò che potrebbe essere perfettamente correttamente, ma potrebbe essere utile toobe un aspetto assicurarsi che i clienti possano ottenere un'esperienza ottimale. Il servizio è possibile definire un set di metriche che possono essere restituiti per scopi di controllo di integrità, ma che non influiscono sul hello bilanciamento delle risorse del cluster di hello. toodo toozero di peso metrico hello, questo set. È consigliabile iniziare tutte le metriche con un peso pari a zero e non aumenta il peso di hello fino a quando non si è certi di aver compreso ponderazione metriche hello influenza bilanciamento delle risorse per il cluster.

> [!TIP]
> Non usare un numero eccessivo di metriche ponderate. Può essere difficile toounderstand perché le istanze del servizio devono essere spostate per bilanciamento del carico. Anche un numero ridotto di metriche può essere molto utile.

Le informazioni che possono indicare hello integrità e le prestazioni dell'applicazione sono un candidato per i report di metrica e l'integrità. Un contatore delle prestazioni della CPU può indicare l'uso di un nodo ma non consente di capire se un servizio specifico sia integro, poiché su quel nodo potrebbero essere in esecuzione più servizi. Ma, metriche come RPS, gli elementi elaborati, e latenza richiesta tutti possa indicare l'integrità di hello di un servizio specifico.

integrità tooreport, utilizzare codice simile toothis:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport una metrica, usare codice simile toothis:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Log di supporto di Service Fabric

Se è necessario toocontact supporto tecnico Microsoft per assistenza con il cluster di Azure Service Fabric, registri di supporto sono quasi sempre necessari. Se il cluster è ospitato in Azure, questi log vengono automaticamente configurati e raccolti in fase di creazione di un cluster. Hello log vengono archiviati in un account di archiviazione dedicati in gruppo di risorse del cluster. account di archiviazione Hello non è un nome predefinito, ma nell'account hello, vedrai contenitori blob e tabelle con nomi che iniziano con *infrastruttura*. Per informazioni sulla configurazione di raccolte di log per un cluster autonomo, vedere [Creare un cluster autonomo di Azure Service Fabric](service-fabric-cluster-creation-for-windows-server.md) e [Impostazioni di configurazione per un cluster autonomo in Windows](service-fabric-cluster-manifest.md). Per le istanze di Service Fabric autonomo, hello log deve essere inviato tooa condivisione di file locale. Si è **obbligatorio** toohave questi log per il supporto, ma non sono previsti toobe utilizzabile da chiunque all'esterno di team di supporto tecnico clienti Microsoft hello.

## <a name="enabling-diagnostics-for-a-cluster"></a>Abilitazione della diagnostica per un cluster

In ordine tootake sfruttare questi registri, si consiglia che durante la creazione del cluster, "Diagnostics" sia abilitata. Attivando la diagnostica, durante la distribuzione hello, diagnostica Windows Azure è in grado di tooacknowledge hello Operational servizi affidabili e canali Reliable actors e archiviare i dati hello come illustrato in maggiore dettaglio nel [aggregare gli eventi con Diagnostica di Azure](service-fabric-diagnostics-event-aggregation-wad.md).

Nell'esempio precedente, è inoltre disponibile un tooadd campo facoltativo, una chiave di strumentazione di Application Insights (AI). Se si sceglie toouse per qualsiasi analisi eventi (ulteriori informazioni in [analisi degli eventi con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), includere risorse manualmente instrumentationKey (GUID) di hello AppInsights qui.


Se si prevede di cluster di tooyour toodeploy contenitori, abilitare toopick WAD le statistiche di docker, aggiungere questo tooyour "WadCfg > DiagnosticMonitorConfiguration":

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Misurazione delle prestazioni

Misurazione delle prestazioni del cluster aiuta a comprendere come è decisioni di carico e delle unità toohandle in grado di sulla scalabilità del cluster (ulteriori informazioni sulla scalabilità di un cluster [in Azure](service-fabric-cluster-scale-up-down.md), o [locale](service-fabric-cluster-windows-server-add-remove-nodes.md)). I dati sulle prestazioni sono inoltre utile quando confrontati tooactions si o le applicazioni e servizi potrebbero avere preso, durante l'analisi del log di hello future. 

Per un elenco di toocollect di contatori delle prestazioni quando si usa Service Fabric, vedere [i contatori delle prestazioni nell'infrastruttura di servizio](service-fabric-diagnostics-event-generation-perf.md)

Di seguito sono illustrati due modi comuni disponibili per configurare la raccolta dei dati sulle prestazioni del cluster.

* Utilizzo di un agente: questo è il metodo hello preferito per la raccolta delle prestazioni da un computer, poiché gli agenti hanno in genere un elenco delle metriche di prestazioni che possono essere raccolti, e è una metrica di un processo relativamente semplice toochoose hello desidera toocollect o modificarli . Conoscenza [come tooconfigure hello OMS per Service Fabric](service-fabric-diagnostics-event-analysis-oms.md) e [impostazione OMS dell'agente di Windows hello](../log-analytics/log-analytics-windows-agents.md) toolearn articoli ulteriori informazioni sull'agente OMS hello, ovvero un tale agente monitoraggio è in grado di toopick dati sulle prestazioni per macchine virtuali del cluster e i contenitori distribuiti.

* Configurazione di diagnostica toowrite prestazioni contatori tabella tooa: per i cluster in Azure, pertanto modifica toopick di configurazione di diagnostica Azure hello dei contatori di prestazioni appropriati hello da hello macchine virtuali del cluster e abilitarlo toopick backup statistiche di docker se si distribuiscono tutti i contenitori. Informazioni di configurazione [contatori delle prestazioni in WAD](service-fabric-diagnostics-event-aggregation-wad.md) in tooset Service Fabric di raccolta contatori delle prestazioni.

## <a name="next-steps"></a>Passaggi successivi

Il log ed eventi necessitano toobe aggregati prima di inviarli tooany piattaforma di analisi. Conoscenza [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprendere alcuni dei hello opzioni consigliata.
