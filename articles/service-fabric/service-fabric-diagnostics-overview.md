---
title: aaaAzure Panoramica di diagnostica e monitoraggio dell'infrastruttura del servizio | Documenti Microsoft
description: Informazioni sul monitoraggio e la diagnostica per i cluster, le applicazioni e i servizi di Azure Service Fabric.
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Monitoraggio e diagnostica in Azure Service Fabric

Monitoraggio e diagnostica è critici toodeveloping, test e distribuzione di applicazioni e servizi in qualsiasi ambiente. Le soluzioni di Service Fabric funzionano meglio quando si pianifica e si implementa il monitoraggio e la diagnostica che consentono di verificare che le applicazioni e i servizi funzionino come previsto in un ambiente di sviluppo locale o in fase di produzione.

Hello obiettivi principali di monitoraggio e la diagnostica:
* Rilevare e diagnosticare i problemi di hardware e infrastruttura
* Rilevare i problemi di software e app, ridurre i tempi di inattività del servizio
* Comprendere l'utilizzo delle risorse e supportare le decisioni operative
* Ottimizzare le prestazioni delle applicazioni, dei servizi e delle infrastrutture
* Generare informazioni aziendali dettagliate e identificare le aree di miglioramento


Hello generale del flusso di lavoro di monitoraggio e diagnostica è costituito da tre passaggi:

1. **Generazione di eventi**: infrastruttura hello (cluster), piattaforma e a livello di applicazione / servizio sono inclusi gli eventi (log, le tracce, gli eventi personalizzati)
2. **Aggregazione evento**: gli eventi generati necessario toobe raccolti e aggregati prima che possano essere visualizzati
3. **Analisi**: gli eventi devono toobe visualizzato e accessibile in un formato, tooallow per l'analisi e visualizzazione in base alle esigenze

Più prodotti sono disponibili che illustrano questi tre aree, se si toochoose libero diverse tecnologie per ognuno. È importante toomake assicurarsi che hello varie parti lavoro insieme toodeliver una soluzione di monitoraggio end-to-end per il cluster.

## <a name="event-generation"></a>Generazione di eventi

Hello hello diagnostica e monitoraggio del flusso di lavoro è innanzitutto hello creazione e generazione di eventi e log. Questi eventi, registri e le tracce vengono generate a due livelli: hello a livello di piattaforma (inclusi i cluster di hello, hello macchine o azioni di Service Fabric) o il livello di applicazione hello (alcuna strumentazione aggiunto tooapps e i servizi installati toohello cluster). Gli eventi di ognuno di questi livelli sono personalizzabili, anche se Service Fabric offre alcuni strumenti per impostazione predefinita.

Altre informazioni sui [eventi a livello di piattaforma](service-fabric-diagnostics-event-generation-infra.md) e [eventi a livello di applicazione](service-fabric-diagnostics-event-generation-app.md) toounderstand quello fornito e come tooadd ulteriormente strumentazione.

Dopo aver apportato una decisione di registrazione del provider che si desidera toouse hello, è necessario toomake che i log vengono aggregati e archiviati correttamente.

## <a name="event-aggregation"></a>Aggregazione di eventi

Per raccogliere i registri di hello e gli eventi generati per le applicazioni e il cluster, in genere consigliabile utilizzare [diagnostica Azure](service-fabric-diagnostics-event-aggregation-wad.md) (raccolta di log basato su tooagent più simile) o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(in-process la raccolta di log).

Raccolta dei log applicazione utilizzando l'estensione di diagnostica di Azure è un'opzione valida per i servizi di Service Fabric se hello set di origini di log e le destinazioni non cambia spesso e viene applicato un mapping diretto tra origini hello e le destinazioni. motivo Hello per questa configurazione di diagnostica Azure avviene a livello di gestione risorse di hello, pertanto la configurazione di toohello modifiche significative che richiede l'aggiornamento/ridistribuire cluster hello. Inoltre, viene usato al meglio per assicurare che i log vengono archiviati in un luogo più permanente, dove è possibile accedervi tramite varie piattaforme di analisi. Ciò significa che è meno efficiente per una pipeline rispetto all'uso di un'opzione come EventFlow.

Utilizzando [EventFlow](https://github.com/Azure/diagnostics-eventflow) consente è servizi toohave inviare i log direttamente analisi tooan e piattaforma di visualizzazione e/o toostorage. Altre librerie (ILogger, Serilog e così via) potrebbero essere utilizzate per hello stesso scopo, ma EventFlow ha il vantaggio di hello di che è stato progettato specificatamente per i servizi Service Fabric insieme e toosupport nel processo log. Questa impostazione tende toohave diversi vantaggi potenziali:

* Facilità di configurazione e distribuzione
    * configurazione di Hello di raccolta dati di diagnostica è solo parte della configurazione del servizio hello. È facile tooalways keep "sincronizzato" con hello il resto dell'applicazione hello
    * È facile ottenere la configurazione per ogni applicazione o servizio
    * La configurazione di destinazioni dei dati tramite EventFlow è semplicemente il pacchetto NuGet appropriato di hello di aggiunta e modifica di hello *eventFlowConfig.json* file
* Flessibilità
    * un'applicazione Hello può inviare dati di hello ogni volta che è necessario toogo, purché vi è una libreria client che supporta il sistema di archiviazione dati hello di destinazione. È possibile aggiungere nuove destinazioni in base alle esigenze
    * È possibile implementare complesse regole di acquisizione, filtro e aggregazione dati
* Contesto e accedere ai dati di applicazione toointernal
    * sottosistema di diagnostica Hello in esecuzione nel processo di applicazioni o servizi hello possibile integrare facilmente le tracce di hello con informazioni contestuali

Una cosa toonote è che queste due opzioni non si escludono a vicenda e durante la possibile tooget un processo simile eseguito con uno o altri hello, potrebbe anche avere senso tooset backup di entrambi. Nella maggior parte dei casi, la combinazione di un agente con l'insieme nel processo provocare tooa più affidabile il monitoraggio del flusso di lavoro. Hello estensione diagnostica di Azure (agente) potrebbe essere scelto un percorso per i log a livello di piattaforma nonostante sia possibile utilizzare EventFlow (in-process insieme) per i log di livello applicazione. Quando hanno realizzato la soluzione più adatta per l'utente, è ora toothink sulla modalità di toobe i dati visualizzati e analizzati.

## <a name="event-analysis"></a>Analisi di eventi

Esistono diverse piattaforme grande che esistono nel mercato hello per quanto riguarda toohello analisi e la visualizzazione dei dati di monitoraggio e diagnostica. Hello consigliati sono due [OMS](service-fabric-diagnostics-event-analysis-oms.md) e [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) scadenza tootheir una migliore integrazione con Service Fabric, ma è consigliabile inoltre esaminare hello [Stack elastico](https://www.elastic.co/products) (in particolare se si sta considerando l'esecuzione di un cluster in un ambiente non in linea), [Splunk](https://www.splunk.com/), o qualsiasi altra piattaforma di preferenza.

Hello punti chiave per qualsiasi piattaforma scelto deve includere come preferisci sono con interfaccia utente di hello e query, opzioni hello dati toovisualize possibilità e creare dashboard facilmente leggibile e hello strumenti aggiuntivi forniscono tooenhance il monitoraggio, ad esempio la notifica automatica.

Inoltre piattaforma toohello che scegliere quando si configura un cluster di Service Fabric come risorsa di Azure, si ottiene anche accesso tooAzure di casella monitoraggio per i computer, che può essere utile per le prestazioni di specifiche e metriche di monitoraggio.

### <a name="azure-monitor"></a>Monitoraggio di Azure

È possibile utilizzare [Monitor Azure](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor molte delle risorse di Azure in cui viene compilato un cluster di Service Fabric di hello. Un set di metriche per hello [set di scalabilità della macchina virtuale](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) e singoli [macchine virtuali](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) vengono automaticamente raccolti e visualizzati nel portale di Azure hello. hello tooview raccolti hello portale di Azure, gruppo di risorse hello select che contiene il cluster di Service Fabric hello di informazioni. Scalabilità della macchina virtuale selezionare hello impostare quindi che si desidera tooview. In hello **monitoraggio** selezionare **metriche** tooview un grafico dei valori hello.

![Visualizzazione del portale di Azure dei dati di metrica raccolti](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

grafici di hello toocustomize, seguire le istruzioni hello [metriche in Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). È anche possibile creare avvisi in base a queste metriche, come illustrato in [Creare avvisi in Monitoraggio di Azure per servizi di Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). È possibile inviare gli avvisi del servizio di notifica tooa tramite hook web, come descritto in [configurare hook web in un avviso di metrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Monitoraggio di Azure supporta solo una sottoscrizione. Se è necessario toomonitor più sottoscrizioni o se sono necessarie ulteriori funzionalità, [Log Analitica](https://azure.microsoft.com/documentation/services/log-analytics/), parte di Microsoft Operations Management Suite, fornisce una soluzione di gestione IT olistica per on-premise e basato su cloud infrastruttura. È possibile indirizzare i dati di monitoraggio di Azure direttamente tooLog Analitica, pertanto è possibile visualizzare le metriche e i log per l'intero ambiente in un'unica posizione.

## <a name="next-steps"></a>Passaggi successivi

### <a name="watchdogs"></a>Watchdog

Un controllo è un servizio separato che può controllare l'integrità e il carico tra servizi e segnalare l'integrità per tutti gli elementi nella gerarchia del modello di integrità hello. Ciò consente di evitare gli errori che non verrebbero rilevati in base a visualizzazione hello di un singolo servizio. Watchdog sono inoltre un codice di toohost buona che esegue le azioni correttive senza interazione dell'utente (ad esempio, pulizia dei file di log nell'archiviazione a determinati intervalli di tempo). È possibile trovare un'implementazione di esempio del servizio watchdog [qui](https://github.com/Azure-Samples/service-fabric-watchdog-service).

Introduzione a comprendere come eventi e log generati in hello [livello piattaforma](service-fabric-diagnostics-event-generation-infra.md) hello e [a livello di applicazione](service-fabric-diagnostics-event-generation-app.md).
